---
title: 'Tutorial: Azure Active Directory integration with FiscalNote | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and FiscalNote.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 55274f26-be7e-4514-964c-7186ecb55c4a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: 2dfc450fe53c543c1d5119cd9c6954aadaa3b3ff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868735"
---
# <a name="tutorial-azure-active-directory-integration-with-fiscalnote"></a><span data-ttu-id="ca05e-103">Tutorial: Azure Active Directory integration with FiscalNote</span><span class="sxs-lookup"><span data-stu-id="ca05e-103">Tutorial: Azure Active Directory integration with FiscalNote</span></span>

<span data-ttu-id="ca05e-104">In this tutorial, you learn how to integrate FiscalNote with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ca05e-104">In this tutorial, you learn how to integrate FiscalNote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ca05e-105">Integrating FiscalNote with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ca05e-105">Integrating FiscalNote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ca05e-106">You can control in Azure AD who has access to FiscalNote.</span><span class="sxs-lookup"><span data-stu-id="ca05e-106">You can control in Azure AD who has access to FiscalNote.</span></span>
- <span data-ttu-id="ca05e-107">You can enable your users to automatically get signed-on to FiscalNote (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="ca05e-107">You can enable your users to automatically get signed-on to FiscalNote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ca05e-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ca05e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ca05e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ca05e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca05e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ca05e-110">Prerequisites</span></span>

<span data-ttu-id="ca05e-111">To configure Azure AD integration with FiscalNote, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ca05e-111">To configure Azure AD integration with FiscalNote, you need the following items:</span></span>

- <span data-ttu-id="ca05e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ca05e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca05e-113">A FiscalNote single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ca05e-113">A FiscalNote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ca05e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ca05e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ca05e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ca05e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca05e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ca05e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ca05e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca05e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca05e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ca05e-118">Scenario description</span></span>
<span data-ttu-id="ca05e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ca05e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ca05e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ca05e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca05e-121">Adding FiscalNote from the gallery</span><span class="sxs-lookup"><span data-stu-id="ca05e-121">Adding FiscalNote from the gallery</span></span>
1. <span data-ttu-id="ca05e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ca05e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fiscalnote-from-the-gallery"></a><span data-ttu-id="ca05e-123">Adding FiscalNote from the gallery</span><span class="sxs-lookup"><span data-stu-id="ca05e-123">Adding FiscalNote from the gallery</span></span>
<span data-ttu-id="ca05e-124">To configure the integration of FiscalNote into Azure AD, you need to add FiscalNote from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ca05e-124">To configure the integration of FiscalNote into Azure AD, you need to add FiscalNote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ca05e-125">**To add FiscalNote from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ca05e-125">**To add FiscalNote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ca05e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ca05e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="ca05e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ca05e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="ca05e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ca05e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="ca05e-133">In the search box, type **FiscalNote**, select **FiscalNote** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ca05e-133">In the search box, type **FiscalNote**, select **FiscalNote** from result panel then click **Add** button to add the application.</span></span>

    ![FiscalNote in the results list](./media/fiscalnote-tutorial/tutorial_fiscalnote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ca05e-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ca05e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ca05e-136">In this section, you configure and test Azure AD single sign-on with FiscalNote based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ca05e-136">In this section, you configure and test Azure AD single sign-on with FiscalNote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ca05e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FiscalNote is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca05e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FiscalNote is to a user in Azure AD.</span></span> <span data-ttu-id="ca05e-138">In other words, a link relationship between an Azure AD user and the related user in FiscalNote needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ca05e-138">In other words, a link relationship between an Azure AD user and the related user in FiscalNote needs to be established.</span></span>

<span data-ttu-id="ca05e-139">To configure and test Azure AD single sign-on with FiscalNote, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ca05e-139">To configure and test Azure AD single sign-on with FiscalNote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ca05e-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ca05e-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ca05e-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca05e-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ca05e-142">**[Create a FiscalNote test user](#create-a-fiscalnote-test-user)** - to have a counterpart of Britta Simon in FiscalNote that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ca05e-142">**[Create a FiscalNote test user](#create-a-fiscalnote-test-user)** - to have a counterpart of Britta Simon in FiscalNote that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="ca05e-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ca05e-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ca05e-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ca05e-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ca05e-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ca05e-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ca05e-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FiscalNote application.</span><span class="sxs-lookup"><span data-stu-id="ca05e-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FiscalNote application.</span></span>

<span data-ttu-id="ca05e-147">**To configure Azure AD single sign-on with FiscalNote, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ca05e-147">**To configure Azure AD single sign-on with FiscalNote, perform the following steps:**</span></span>

1. <span data-ttu-id="ca05e-148">In the Azure portal, on the **FiscalNote** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-148">In the Azure portal, on the **FiscalNote** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="ca05e-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ca05e-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/fiscalnote-tutorial/tutorial_fiscalnote_samlbase.png)

1. <span data-ttu-id="ca05e-152">On the **FiscalNote Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ca05e-152">On the **FiscalNote Domain and URLs** section, perform the following steps:</span></span>

    ![FiscalNote Domain and URLs single sign-on information](./media/fiscalnote-tutorial/tutorial_fiscalnote_url.png)
    
    <span data-ttu-id="ca05e-154">a.</span><span class="sxs-lookup"><span data-stu-id="ca05e-154">a.</span></span> <span data-ttu-id="ca05e-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<InstanceName>.fiscalnote.com/login?client=<ClientID>&redirect_uri=https://app.fiscalnote.com/saml-login.html&audience=https://api.fiscalnote.com/&connection=<CONNECTION_NAME>&response_type=id_token%20token`</span><span class="sxs-lookup"><span data-stu-id="ca05e-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<InstanceName>.fiscalnote.com/login?client=<ClientID>&redirect_uri=https://app.fiscalnote.com/saml-login.html&audience=https://api.fiscalnote.com/&connection=<CONNECTION_NAME>&response_type=id_token%20token`</span></span>

    <span data-ttu-id="ca05e-156">b.</span><span class="sxs-lookup"><span data-stu-id="ca05e-156">b.</span></span> <span data-ttu-id="ca05e-157">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:fiscalnote:<CONNECTIONNAME>`</span><span class="sxs-lookup"><span data-stu-id="ca05e-157">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:fiscalnote:<CONNECTIONNAME>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca05e-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="ca05e-158">These values are not real.</span></span> <span data-ttu-id="ca05e-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="ca05e-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ca05e-160">Contact [FiscalNote Client support team](mailto:support@fiscalnote.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="ca05e-160">Contact [FiscalNote Client support team](mailto:support@fiscalnote.com) to get these values.</span></span>

1. <span data-ttu-id="ca05e-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ca05e-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/fiscalnote-tutorial/tutorial_fiscalnote_certificate.png)

1. <span data-ttu-id="ca05e-163">The FiscalNote application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="ca05e-163">The FiscalNote application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ca05e-164">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="ca05e-164">Configure the following claims for this application.</span></span> <span data-ttu-id="ca05e-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="ca05e-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span>

    ![Configure Single Sign-On](./media/fiscalnote-tutorial/tutorial_attribute.png)

1. <span data-ttu-id="ca05e-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ca05e-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
           
    | <span data-ttu-id="ca05e-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="ca05e-168">Attribute Name</span></span> | <span data-ttu-id="ca05e-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="ca05e-169">Attribute Value</span></span> |
    | ---------------| ----------------|
    | <span data-ttu-id="ca05e-170">name</span><span class="sxs-lookup"><span data-stu-id="ca05e-170">name</span></span> | <span data-ttu-id="ca05e-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ca05e-171">user.userprincipalname</span></span>|
    | <span data-ttu-id="ca05e-172">givenName</span><span class="sxs-lookup"><span data-stu-id="ca05e-172">givenName</span></span>| <span data-ttu-id="ca05e-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ca05e-173">user.givenname</span></span>|
    | <span data-ttu-id="ca05e-174">familyName</span><span class="sxs-lookup"><span data-stu-id="ca05e-174">familyName</span></span>| <span data-ttu-id="ca05e-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="ca05e-175">user.surname</span></span>|
    | <span data-ttu-id="ca05e-176">email</span><span class="sxs-lookup"><span data-stu-id="ca05e-176">email</span></span>| <span data-ttu-id="ca05e-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="ca05e-177">user.mail</span></span>|
    
    <span data-ttu-id="ca05e-178">a.</span><span class="sxs-lookup"><span data-stu-id="ca05e-178">a.</span></span> <span data-ttu-id="ca05e-179">Remove existing attributes and add new attributes.</span><span class="sxs-lookup"><span data-stu-id="ca05e-179">Remove existing attributes and add new attributes.</span></span> <span data-ttu-id="ca05e-180">Click on **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="ca05e-180">Click on **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/fiscalnote-tutorial/tutorial_attribute_04.png)
    
    ![Configure Single Sign-On](./media/fiscalnote-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ca05e-183">b.</span><span class="sxs-lookup"><span data-stu-id="ca05e-183">b.</span></span> <span data-ttu-id="ca05e-184">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ca05e-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="ca05e-185">c.</span><span class="sxs-lookup"><span data-stu-id="ca05e-185">c.</span></span> <span data-ttu-id="ca05e-186">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ca05e-186">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="ca05e-187">d.</span><span class="sxs-lookup"><span data-stu-id="ca05e-187">d.</span></span> <span data-ttu-id="ca05e-188">Leave namespace as blank.</span><span class="sxs-lookup"><span data-stu-id="ca05e-188">Leave namespace as blank.</span></span>
    
    <span data-ttu-id="ca05e-189">e.</span><span class="sxs-lookup"><span data-stu-id="ca05e-189">e.</span></span> <span data-ttu-id="ca05e-190">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-190">Click **Ok**.</span></span>

1. <span data-ttu-id="ca05e-191">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ca05e-191">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/fiscalnote-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="ca05e-193">On the **FiscalNote Configuration** section, click **Configure FiscalNote** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="ca05e-193">On the **FiscalNote Configuration** section, click **Configure FiscalNote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ca05e-194">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="ca05e-194">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![FiscalNote Configuration](./media/fiscalnote-tutorial/tutorial_fiscalnote_configure.png) 

1. <span data-ttu-id="ca05e-196">To configure single sign-on on **FiscalNote** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [FiscalNote support team](mailto:support@fiscalnote.com).</span><span class="sxs-lookup"><span data-stu-id="ca05e-196">To configure single sign-on on **FiscalNote** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [FiscalNote support team](mailto:support@fiscalnote.com).</span></span> <span data-ttu-id="ca05e-197">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="ca05e-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ca05e-198">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ca05e-198">Create an Azure AD test user</span></span>

<span data-ttu-id="ca05e-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca05e-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="ca05e-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ca05e-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ca05e-202">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="ca05e-202">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/fiscalnote-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="ca05e-204">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-204">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/fiscalnote-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="ca05e-206">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ca05e-206">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/fiscalnote-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="ca05e-208">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ca05e-208">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/fiscalnote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ca05e-210">a.</span><span class="sxs-lookup"><span data-stu-id="ca05e-210">a.</span></span> <span data-ttu-id="ca05e-211">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-211">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca05e-212">b.</span><span class="sxs-lookup"><span data-stu-id="ca05e-212">b.</span></span> <span data-ttu-id="ca05e-213">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca05e-213">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ca05e-214">c.</span><span class="sxs-lookup"><span data-stu-id="ca05e-214">c.</span></span> <span data-ttu-id="ca05e-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="ca05e-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ca05e-216">d.</span><span class="sxs-lookup"><span data-stu-id="ca05e-216">d.</span></span> <span data-ttu-id="ca05e-217">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-217">Click **Create**.</span></span>
 
### <a name="create-a-fiscalnote-test-user"></a><span data-ttu-id="ca05e-218">Create a FiscalNote test user</span><span class="sxs-lookup"><span data-stu-id="ca05e-218">Create a FiscalNote test user</span></span>

<span data-ttu-id="ca05e-219">The objective of this section is to create a user called Britta Simon in FiscalNote.</span><span class="sxs-lookup"><span data-stu-id="ca05e-219">The objective of this section is to create a user called Britta Simon in FiscalNote.</span></span> <span data-ttu-id="ca05e-220">FiscalNote supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="ca05e-220">FiscalNote supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="ca05e-221">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="ca05e-221">There is no action item for you in this section.</span></span> <span data-ttu-id="ca05e-222">A new user is created during an attempt to access FiscalNote if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="ca05e-222">A new user is created during an attempt to access FiscalNote if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="ca05e-223">If you need to create a user manually, contact [FiscalNote support team](mailto:support@fiscalnote.com).</span><span class="sxs-lookup"><span data-stu-id="ca05e-223">If you need to create a user manually, contact [FiscalNote support team](mailto:support@fiscalnote.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ca05e-224">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ca05e-224">Assign the Azure AD test user</span></span>

<span data-ttu-id="ca05e-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FiscalNote.</span><span class="sxs-lookup"><span data-stu-id="ca05e-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FiscalNote.</span></span>

![Assign the user role][200] 

<span data-ttu-id="ca05e-227">**To assign Britta Simon to FiscalNote, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ca05e-227">**To assign Britta Simon to FiscalNote, perform the following steps:**</span></span>

1. <span data-ttu-id="ca05e-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="ca05e-230">In the applications list, select **FiscalNote**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-230">In the applications list, select **FiscalNote**.</span></span>

    ![The FiscalNote link in the Applications list](./media/fiscalnote-tutorial/tutorial_fiscalnote_app.png)  

1. <span data-ttu-id="ca05e-232">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ca05e-232">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="ca05e-234">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ca05e-234">Click **Add** button.</span></span> <span data-ttu-id="ca05e-235">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ca05e-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="ca05e-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ca05e-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ca05e-238">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ca05e-238">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ca05e-239">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ca05e-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ca05e-240">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ca05e-240">Test single sign-on</span></span>

<span data-ttu-id="ca05e-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ca05e-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ca05e-242">When you click the FiscalNote tile in the Access Panel, you should get automatically signed-on to your FiscalNote application.</span><span class="sxs-lookup"><span data-stu-id="ca05e-242">When you click the FiscalNote tile in the Access Panel, you should get automatically signed-on to your FiscalNote application.</span></span>
<span data-ttu-id="ca05e-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca05e-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ca05e-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ca05e-244">Additional resources</span></span>

* [<span data-ttu-id="ca05e-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca05e-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ca05e-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ca05e-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/fiscalnote-tutorial/tutorial_general_01.png
[2]: ./media/fiscalnote-tutorial/tutorial_general_02.png
[3]: ./media/fiscalnote-tutorial/tutorial_general_03.png
[4]: ./media/fiscalnote-tutorial/tutorial_general_04.png

[100]: ./media/fiscalnote-tutorial/tutorial_general_100.png

[200]: ./media/fiscalnote-tutorial/tutorial_general_200.png
[201]: ./media/fiscalnote-tutorial/tutorial_general_201.png
[202]: ./media/fiscalnote-tutorial/tutorial_general_202.png
[203]: ./media/fiscalnote-tutorial/tutorial_general_203.png

