---
title: 'Tutorial: Azure Active Directory integration with Apptio | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Apptio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: b23eba91-7698-47e7-ae75-0ceafd739965
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/6/2017
ms.author: jeedes
ms.openlocfilehash: ad5c8a61a83211147f5e4929a4f4f6fab738ba32
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871123"
---
# <a name="tutorial-azure-active-directory-integration-with-apptio"></a><span data-ttu-id="86aca-103">Tutorial: Azure Active Directory integration with Apptio</span><span class="sxs-lookup"><span data-stu-id="86aca-103">Tutorial: Azure Active Directory integration with Apptio</span></span>

<span data-ttu-id="86aca-104">In this tutorial, you learn how to integrate Apptio with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86aca-104">In this tutorial, you learn how to integrate Apptio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86aca-105">Integrating Apptio with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="86aca-105">Integrating Apptio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="86aca-106">You can control in Azure AD who has access to Apptio.</span><span class="sxs-lookup"><span data-stu-id="86aca-106">You can control in Azure AD who has access to Apptio.</span></span>
- <span data-ttu-id="86aca-107">You can enable your users to automatically get signed-on to Apptio (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="86aca-107">You can enable your users to automatically get signed-on to Apptio (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="86aca-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="86aca-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="86aca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="86aca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86aca-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="86aca-110">Prerequisites</span></span>

<span data-ttu-id="86aca-111">To configure Azure AD integration with Apptio, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="86aca-111">To configure Azure AD integration with Apptio, you need the following items:</span></span>

- <span data-ttu-id="86aca-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="86aca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86aca-113">An Apptio single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="86aca-113">An Apptio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86aca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="86aca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86aca-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="86aca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86aca-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="86aca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86aca-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86aca-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86aca-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="86aca-118">Scenario description</span></span>
<span data-ttu-id="86aca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="86aca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86aca-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="86aca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86aca-121">Adding Apptio from the gallery</span><span class="sxs-lookup"><span data-stu-id="86aca-121">Adding Apptio from the gallery</span></span>
2. <span data-ttu-id="86aca-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="86aca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-apptio-from-the-gallery"></a><span data-ttu-id="86aca-123">Adding Apptio from the gallery</span><span class="sxs-lookup"><span data-stu-id="86aca-123">Adding Apptio from the gallery</span></span>
<span data-ttu-id="86aca-124">To configure the integration of Apptio into Azure AD, you need to add Apptio from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="86aca-124">To configure the integration of Apptio into Azure AD, you need to add Apptio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="86aca-125">**To add Apptio from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="86aca-125">**To add Apptio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="86aca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="86aca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="86aca-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="86aca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="86aca-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="86aca-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="86aca-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="86aca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="86aca-133">In the search box, type **Apptio**, select **Apptio** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="86aca-133">In the search box, type **Apptio**, select **Apptio** from result panel then click **Add** button to add the application.</span></span>

    ![Apptio in the results list](./media/apptio-tutorial/tutorial_apptio_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="86aca-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="86aca-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="86aca-136">In this section, you configure and test Azure AD single sign-on with Apptio based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="86aca-136">In this section, you configure and test Azure AD single sign-on with Apptio based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="86aca-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Apptio is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86aca-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Apptio is to a user in Azure AD.</span></span> <span data-ttu-id="86aca-138">In other words, a link relationship between an Azure AD user and the related user in Apptio needs to be established.</span><span class="sxs-lookup"><span data-stu-id="86aca-138">In other words, a link relationship between an Azure AD user and the related user in Apptio needs to be established.</span></span>

<span data-ttu-id="86aca-139">In Apptio, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="86aca-139">In Apptio, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="86aca-140">To configure and test Azure AD single sign-on with Apptio, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="86aca-140">To configure and test Azure AD single sign-on with Apptio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="86aca-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="86aca-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="86aca-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86aca-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86aca-143">**[Create an Apptio test user](#create-an-apptio-test-user)** - to have a counterpart of Britta Simon in Apptio that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="86aca-143">**[Create an Apptio test user](#create-an-apptio-test-user)** - to have a counterpart of Britta Simon in Apptio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="86aca-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="86aca-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86aca-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="86aca-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="86aca-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="86aca-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="86aca-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Apptio application.</span><span class="sxs-lookup"><span data-stu-id="86aca-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Apptio application.</span></span>

<span data-ttu-id="86aca-148">**To configure Azure AD single sign-on with Apptio, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="86aca-148">**To configure Azure AD single sign-on with Apptio, perform the following steps:**</span></span>

1. <span data-ttu-id="86aca-149">In the Azure portal, on the **Apptio** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="86aca-149">In the Azure portal, on the **Apptio** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="86aca-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="86aca-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/apptio-tutorial/tutorial_apptio_samlbase.png)

3. <span data-ttu-id="86aca-153">On the **Apptio Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="86aca-153">On the **Apptio Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Apptio Domain and URLs single sign-on information](./media/apptio-tutorial/tutorial_apptio_url.png)

    <span data-ttu-id="86aca-155">In the **Identifier** textbox, type the value: `urn:federation:apptio`</span><span class="sxs-lookup"><span data-stu-id="86aca-155">In the **Identifier** textbox, type the value: `urn:federation:apptio`</span></span>

4. <span data-ttu-id="86aca-156">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="86aca-156">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/apptio-tutorial/tutorial_apptio_certificate.png) 

5. <span data-ttu-id="86aca-158">The Apptio Software application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="86aca-158">The Apptio Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="86aca-159">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="86aca-159">Please configure the following claims for this application.</span></span> <span data-ttu-id="86aca-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="86aca-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="86aca-161">Please note that **User Identifier** is mapped with **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="86aca-161">Please note that **User Identifier** is mapped with **user.mail**.</span></span> <span data-ttu-id="86aca-162">There are other three attributes - **fullname, mail and role** which you need to configure.</span><span class="sxs-lookup"><span data-stu-id="86aca-162">There are other three attributes - **fullname, mail and role** which you need to configure.</span></span> <span data-ttu-id="86aca-163">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="86aca-163">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/apptio-tutorial/tutorial_apptio_attributes.png)     
    
    > [!NOTE]
    > <span data-ttu-id="86aca-165">Please click [here](../../role-based-access-control/role-assignments-portal.md) to know how to configure **Role** in Azure AD</span><span class="sxs-lookup"><span data-stu-id="86aca-165">Please click [here](../../role-based-access-control/role-assignments-portal.md) to know how to configure **Role** in Azure AD</span></span>
    
6. <span data-ttu-id="86aca-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="86aca-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>

    | <span data-ttu-id="86aca-167">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="86aca-167">Attribute Name</span></span> | <span data-ttu-id="86aca-168">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="86aca-168">Attribute Value</span></span> |
    | -------------- | -------------------- |    
    | <span data-ttu-id="86aca-169">fullname</span><span class="sxs-lookup"><span data-stu-id="86aca-169">fullname</span></span>       | <span data-ttu-id="86aca-170">user.displayname</span><span class="sxs-lookup"><span data-stu-id="86aca-170">user.displayname</span></span> |
    | <span data-ttu-id="86aca-171">mail</span><span class="sxs-lookup"><span data-stu-id="86aca-171">mail</span></span>           | <span data-ttu-id="86aca-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="86aca-172">user.mail</span></span> |
    | <span data-ttu-id="86aca-173">role</span><span class="sxs-lookup"><span data-stu-id="86aca-173">role</span></span>           | <span data-ttu-id="86aca-174">user.assignedrole</span><span class="sxs-lookup"><span data-stu-id="86aca-174">user.assignedrole</span></span> |
    
    <span data-ttu-id="86aca-175">a.</span><span class="sxs-lookup"><span data-stu-id="86aca-175">a.</span></span> <span data-ttu-id="86aca-176">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="86aca-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/apptio-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/apptio-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="86aca-179">b.</span><span class="sxs-lookup"><span data-stu-id="86aca-179">b.</span></span> <span data-ttu-id="86aca-180">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="86aca-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="86aca-181">c.</span><span class="sxs-lookup"><span data-stu-id="86aca-181">c.</span></span> <span data-ttu-id="86aca-182">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="86aca-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="86aca-183">d.</span><span class="sxs-lookup"><span data-stu-id="86aca-183">d.</span></span> <span data-ttu-id="86aca-184">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="86aca-184">Click **Ok**.</span></span>

8. <span data-ttu-id="86aca-185">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="86aca-185">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/apptio-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="86aca-187">To configure single sign-on on **Apptio** side, you need to send the downloaded **Metadata XML** to [Apptio support team](https://www.apptio.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="86aca-187">To configure single sign-on on **Apptio** side, you need to send the downloaded **Metadata XML** to [Apptio support team](https://www.apptio.com/about/contact).</span></span> <span data-ttu-id="86aca-188">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="86aca-188">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="86aca-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="86aca-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="86aca-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="86aca-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="86aca-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86aca-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="86aca-192">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="86aca-192">Create an Azure AD test user</span></span>

<span data-ttu-id="86aca-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86aca-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="86aca-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="86aca-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="86aca-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="86aca-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/apptio-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="86aca-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="86aca-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/apptio-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="86aca-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="86aca-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/apptio-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="86aca-202">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="86aca-202">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/apptio-tutorial/create_aaduser_04.png)

    <span data-ttu-id="86aca-204">a.</span><span class="sxs-lookup"><span data-stu-id="86aca-204">a.</span></span> <span data-ttu-id="86aca-205">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86aca-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86aca-206">b.</span><span class="sxs-lookup"><span data-stu-id="86aca-206">b.</span></span> <span data-ttu-id="86aca-207">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86aca-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="86aca-208">c.</span><span class="sxs-lookup"><span data-stu-id="86aca-208">c.</span></span> <span data-ttu-id="86aca-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="86aca-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="86aca-210">d.</span><span class="sxs-lookup"><span data-stu-id="86aca-210">d.</span></span> <span data-ttu-id="86aca-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="86aca-211">Click **Create**.</span></span>
 
### <a name="create-an-apptio-test-user"></a><span data-ttu-id="86aca-212">Create an Apptio test user</span><span class="sxs-lookup"><span data-stu-id="86aca-212">Create an Apptio test user</span></span>

<span data-ttu-id="86aca-213">In this section, you create a user called Britta Simon in Apptio.</span><span class="sxs-lookup"><span data-stu-id="86aca-213">In this section, you create a user called Britta Simon in Apptio.</span></span> <span data-ttu-id="86aca-214">Work with [Apptio support team](https://www.apptio.com/about/contact) to add the users in the Apptio platform.</span><span class="sxs-lookup"><span data-stu-id="86aca-214">Work with [Apptio support team](https://www.apptio.com/about/contact) to add the users in the Apptio platform.</span></span> <span data-ttu-id="86aca-215">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="86aca-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="86aca-216">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="86aca-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="86aca-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Apptio.</span><span class="sxs-lookup"><span data-stu-id="86aca-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Apptio.</span></span>

![Assign the user role][200] 

<span data-ttu-id="86aca-219">**To assign Britta Simon to Apptio, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="86aca-219">**To assign Britta Simon to Apptio, perform the following steps:**</span></span>

1. <span data-ttu-id="86aca-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="86aca-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="86aca-222">In the applications list, select **Apptio**.</span><span class="sxs-lookup"><span data-stu-id="86aca-222">In the applications list, select **Apptio**.</span></span>

    ![The Apptio link in the Applications list](./media/apptio-tutorial/tutorial_apptio_app.png)  

3. <span data-ttu-id="86aca-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="86aca-224">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="86aca-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="86aca-226">Click **Add** button.</span></span> <span data-ttu-id="86aca-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="86aca-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="86aca-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="86aca-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="86aca-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="86aca-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86aca-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="86aca-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="86aca-232">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="86aca-232">Test single sign-on</span></span>

<span data-ttu-id="86aca-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="86aca-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="86aca-234">When you click the Apptio tile in the Access Panel, you should get automatically signed-on to your Apptio application.</span><span class="sxs-lookup"><span data-stu-id="86aca-234">When you click the Apptio tile in the Access Panel, you should get automatically signed-on to your Apptio application.</span></span>
<span data-ttu-id="86aca-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="86aca-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="86aca-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="86aca-236">Additional resources</span></span>

* [<span data-ttu-id="86aca-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86aca-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="86aca-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86aca-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/apptio-tutorial/tutorial_general_01.png
[2]: ./media/apptio-tutorial/tutorial_general_02.png
[3]: ./media/apptio-tutorial/tutorial_general_03.png
[4]: ./media/apptio-tutorial/tutorial_general_04.png

[100]: ./media/apptio-tutorial/tutorial_general_100.png

[200]: ./media/apptio-tutorial/tutorial_general_200.png
[201]: ./media/apptio-tutorial/tutorial_general_201.png
[202]: ./media/apptio-tutorial/tutorial_general_202.png
[203]: ./media/apptio-tutorial/tutorial_general_203.png
