---
title: 'Tutorial: Azure Active Directory integration with AppNeta Performance Monitor | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and AppNeta Performance Monitor.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 643a45fb-d6fc-4b32-b721-68899f8c7d44
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2018
ms.author: jeedes
ms.openlocfilehash: ccedc0288e313df2639862a14078d8cad9951286
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867585"
---
# <a name="tutorial-azure-active-directory-integration-with-appneta-performance-monitor"></a><span data-ttu-id="9500c-103">Tutorial: Azure Active Directory integration with AppNeta Performance Monitor</span><span class="sxs-lookup"><span data-stu-id="9500c-103">Tutorial: Azure Active Directory integration with AppNeta Performance Monitor</span></span>

<span data-ttu-id="9500c-104">In this tutorial, you learn how to integrate AppNeta Performance Monitor with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9500c-104">In this tutorial, you learn how to integrate AppNeta Performance Monitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9500c-105">Integrating AppNeta Performance Monitor with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9500c-105">Integrating AppNeta Performance Monitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9500c-106">You can control in Azure AD who has access to AppNeta Performance Monitor.</span><span class="sxs-lookup"><span data-stu-id="9500c-106">You can control in Azure AD who has access to AppNeta Performance Monitor.</span></span>
- <span data-ttu-id="9500c-107">You can enable your users to automatically get signed-on to AppNeta Performance Monitor (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="9500c-107">You can enable your users to automatically get signed-on to AppNeta Performance Monitor (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9500c-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9500c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9500c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9500c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9500c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9500c-110">Prerequisites</span></span>

<span data-ttu-id="9500c-111">To configure Azure AD integration with AppNeta Performance Monitor, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9500c-111">To configure Azure AD integration with AppNeta Performance Monitor, you need the following items:</span></span>

- <span data-ttu-id="9500c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9500c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9500c-113">An AppNeta Performance Monitor single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9500c-113">An AppNeta Performance Monitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9500c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9500c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9500c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9500c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9500c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9500c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9500c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9500c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9500c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9500c-118">Scenario description</span></span>
<span data-ttu-id="9500c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9500c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9500c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9500c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9500c-121">Adding AppNeta Performance Monitor from the gallery</span><span class="sxs-lookup"><span data-stu-id="9500c-121">Adding AppNeta Performance Monitor from the gallery</span></span>
2. <span data-ttu-id="9500c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9500c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appneta-performance-monitor-from-the-gallery"></a><span data-ttu-id="9500c-123">Adding AppNeta Performance Monitor from the gallery</span><span class="sxs-lookup"><span data-stu-id="9500c-123">Adding AppNeta Performance Monitor from the gallery</span></span>
<span data-ttu-id="9500c-124">To configure the integration of AppNeta Performance Monitor into Azure AD, you need to add AppNeta Performance Monitor from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9500c-124">To configure the integration of AppNeta Performance Monitor into Azure AD, you need to add AppNeta Performance Monitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9500c-125">**To add AppNeta Performance Monitor from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9500c-125">**To add AppNeta Performance Monitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9500c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9500c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="9500c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9500c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9500c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9500c-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="9500c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9500c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="9500c-133">In the search box, type **AppNeta Performance Monitor**, select **AppNeta Performance Monitor** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9500c-133">In the search box, type **AppNeta Performance Monitor**, select **AppNeta Performance Monitor** from result panel then click **Add** button to add the application.</span></span>

    ![AppNeta Performance Monitor in the results list](./media/appneta-tutorial/tutorial_appneta_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9500c-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9500c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9500c-136">In this section, you configure and test Azure AD single sign-on with AppNeta Performance Monitor based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9500c-136">In this section, you configure and test Azure AD single sign-on with AppNeta Performance Monitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9500c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in AppNeta Performance Monitor is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9500c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in AppNeta Performance Monitor is to a user in Azure AD.</span></span> <span data-ttu-id="9500c-138">In other words, a link relationship between an Azure AD user and the related user in AppNeta Performance Monitor needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9500c-138">In other words, a link relationship between an Azure AD user and the related user in AppNeta Performance Monitor needs to be established.</span></span>

<span data-ttu-id="9500c-139">To configure and test Azure AD single sign-on with AppNeta Performance Monitor, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9500c-139">To configure and test Azure AD single sign-on with AppNeta Performance Monitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9500c-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9500c-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9500c-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9500c-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9500c-142">**[Create an AppNeta Performance Monitor test user](#create-an-appneta-performance-monitor-test-user)** - to have a counterpart of Britta Simon in AppNeta Performance Monitor that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9500c-142">**[Create an AppNeta Performance Monitor test user](#create-an-appneta-performance-monitor-test-user)** - to have a counterpart of Britta Simon in AppNeta Performance Monitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9500c-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9500c-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9500c-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9500c-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9500c-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9500c-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9500c-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppNeta Performance Monitor application.</span><span class="sxs-lookup"><span data-stu-id="9500c-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppNeta Performance Monitor application.</span></span>

<span data-ttu-id="9500c-147">**To configure Azure AD single sign-on with AppNeta Performance Monitor, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9500c-147">**To configure Azure AD single sign-on with AppNeta Performance Monitor, perform the following steps:**</span></span>

1. <span data-ttu-id="9500c-148">In the Azure portal, on the **AppNeta Performance Monitor** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9500c-148">In the Azure portal, on the **AppNeta Performance Monitor** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="9500c-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9500c-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/appneta-tutorial/tutorial_appneta_samlbase.png)

3. <span data-ttu-id="9500c-152">On the **AppNeta Performance Monitor Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9500c-152">On the **AppNeta Performance Monitor Domain and URLs** section, perform the following steps:</span></span>

    ![AppNeta Performance Monitor Domain and URLs single sign-on information](./media/appneta-tutorial/tutorial_appneta_url.png)

    <span data-ttu-id="9500c-154">a.</span><span class="sxs-lookup"><span data-stu-id="9500c-154">a.</span></span> <span data-ttu-id="9500c-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.pm.appneta.com`</span><span class="sxs-lookup"><span data-stu-id="9500c-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.pm.appneta.com`</span></span>

    <span data-ttu-id="9500c-156">b.</span><span class="sxs-lookup"><span data-stu-id="9500c-156">b.</span></span> <span data-ttu-id="9500c-157">In the **Identifier** textbox, type the value: `PingConnect`</span><span class="sxs-lookup"><span data-stu-id="9500c-157">In the **Identifier** textbox, type the value: `PingConnect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9500c-158">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="9500c-158">The Sign-on URL value is not real.</span></span> <span data-ttu-id="9500c-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="9500c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="9500c-160">Contact [AppNeta Performance Monitor Client support team](mailto:support@appneta.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="9500c-160">Contact [AppNeta Performance Monitor Client support team](mailto:support@appneta.com) to get this value.</span></span> 

5. <span data-ttu-id="9500c-161">The AppNeta Performance Monitor application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="9500c-161">The AppNeta Performance Monitor application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="9500c-162">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="9500c-162">Configure the following claims for this application.</span></span> <span data-ttu-id="9500c-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="9500c-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span>

    ![Configure Single Sign-On](./media/appneta-tutorial/attribute.png)

6. <span data-ttu-id="9500c-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9500c-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
           
    | <span data-ttu-id="9500c-166">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="9500c-166">Attribute Name</span></span> | <span data-ttu-id="9500c-167">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="9500c-167">Attribute Value</span></span> |
    | ---------------| ----------------|
    | <span data-ttu-id="9500c-168">firstName</span><span class="sxs-lookup"><span data-stu-id="9500c-168">firstName</span></span>| <span data-ttu-id="9500c-169">user.givenname</span><span class="sxs-lookup"><span data-stu-id="9500c-169">user.givenname</span></span>|
    | <span data-ttu-id="9500c-170">lastName</span><span class="sxs-lookup"><span data-stu-id="9500c-170">lastName</span></span>| <span data-ttu-id="9500c-171">user.surname</span><span class="sxs-lookup"><span data-stu-id="9500c-171">user.surname</span></span>|
    | <span data-ttu-id="9500c-172">email</span><span class="sxs-lookup"><span data-stu-id="9500c-172">email</span></span>| <span data-ttu-id="9500c-173">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="9500c-173">user.userprincipalname</span></span>|
    | <span data-ttu-id="9500c-174">name</span><span class="sxs-lookup"><span data-stu-id="9500c-174">name</span></span>| <span data-ttu-id="9500c-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="9500c-175">user.userprincipalname</span></span>|
    | <span data-ttu-id="9500c-176">groups</span><span class="sxs-lookup"><span data-stu-id="9500c-176">groups</span></span>   | <span data-ttu-id="9500c-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="9500c-177">user.assignedroles</span></span> |
    | <span data-ttu-id="9500c-178">phone</span><span class="sxs-lookup"><span data-stu-id="9500c-178">phone</span></span>| <span data-ttu-id="9500c-179">user.telephonenumber</span><span class="sxs-lookup"><span data-stu-id="9500c-179">user.telephonenumber</span></span> |
    | <span data-ttu-id="9500c-180">title</span><span class="sxs-lookup"><span data-stu-id="9500c-180">title</span></span>| <span data-ttu-id="9500c-181">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="9500c-181">user.jobtitle</span></span>|

    > [!NOTE]
    > <span data-ttu-id="9500c-182">'groups' refers to the security group in Appneta which is mapped to a 'Role' in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9500c-182">'groups' refers to the security group in Appneta which is mapped to a 'Role' in Azure AD.</span></span> <span data-ttu-id="9500c-183">Please refer to [this](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-app-role-management) doc which explains how to create custom roles in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9500c-183">Please refer to [this](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-app-role-management) doc which explains how to create custom roles in Azure AD.</span></span>
        
    <span data-ttu-id="9500c-184">a.</span><span class="sxs-lookup"><span data-stu-id="9500c-184">a.</span></span> <span data-ttu-id="9500c-185">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="9500c-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/appneta-tutorial/tutorial_attribute_04.png)
    
    ![Configure Single Sign-On](./media/appneta-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9500c-188">b.</span><span class="sxs-lookup"><span data-stu-id="9500c-188">b.</span></span> <span data-ttu-id="9500c-189">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="9500c-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="9500c-190">c.</span><span class="sxs-lookup"><span data-stu-id="9500c-190">c.</span></span> <span data-ttu-id="9500c-191">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="9500c-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="9500c-192">d.</span><span class="sxs-lookup"><span data-stu-id="9500c-192">d.</span></span> <span data-ttu-id="9500c-193">Leave namespace as blank.</span><span class="sxs-lookup"><span data-stu-id="9500c-193">Leave namespace as blank.</span></span>
    
    <span data-ttu-id="9500c-194">e.</span><span class="sxs-lookup"><span data-stu-id="9500c-194">e.</span></span> <span data-ttu-id="9500c-195">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="9500c-195">Click **Ok**.</span></span>  

4. <span data-ttu-id="9500c-196">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9500c-196">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/appneta-tutorial/tutorial_appneta_certificate.png) 

5. <span data-ttu-id="9500c-198">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9500c-198">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/appneta-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9500c-200">To configure single sign-on on **AppNeta Performance Monitor** side, you need to send the downloaded **Metadata XML** to [AppNeta Performance Monitor support team](mailto:support@appneta.com).</span><span class="sxs-lookup"><span data-stu-id="9500c-200">To configure single sign-on on **AppNeta Performance Monitor** side, you need to send the downloaded **Metadata XML** to [AppNeta Performance Monitor support team](mailto:support@appneta.com).</span></span> <span data-ttu-id="9500c-201">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="9500c-201">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9500c-202">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9500c-202">Create an Azure AD test user</span></span>

<span data-ttu-id="9500c-203">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9500c-203">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="9500c-205">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9500c-205">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9500c-206">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="9500c-206">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/appneta-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9500c-208">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9500c-208">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/appneta-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9500c-210">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="9500c-210">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/appneta-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9500c-212">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9500c-212">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/appneta-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9500c-214">a.</span><span class="sxs-lookup"><span data-stu-id="9500c-214">a.</span></span> <span data-ttu-id="9500c-215">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9500c-215">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9500c-216">b.</span><span class="sxs-lookup"><span data-stu-id="9500c-216">b.</span></span> <span data-ttu-id="9500c-217">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9500c-217">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9500c-218">c.</span><span class="sxs-lookup"><span data-stu-id="9500c-218">c.</span></span> <span data-ttu-id="9500c-219">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="9500c-219">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9500c-220">d.</span><span class="sxs-lookup"><span data-stu-id="9500c-220">d.</span></span> <span data-ttu-id="9500c-221">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9500c-221">Click **Create**.</span></span>
 
### <a name="create-an-appneta-performance-monitor-test-user"></a><span data-ttu-id="9500c-222">Create an AppNeta Performance Monitor test user</span><span class="sxs-lookup"><span data-stu-id="9500c-222">Create an AppNeta Performance Monitor test user</span></span>

<span data-ttu-id="9500c-223">The objective of this section is to create a user called Britta Simon in AppNeta Performance Monitor.</span><span class="sxs-lookup"><span data-stu-id="9500c-223">The objective of this section is to create a user called Britta Simon in AppNeta Performance Monitor.</span></span> <span data-ttu-id="9500c-224">AppNeta Performance Monitor supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="9500c-224">AppNeta Performance Monitor supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="9500c-225">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="9500c-225">There is no action item for you in this section.</span></span> <span data-ttu-id="9500c-226">A new user is created during an attempt to access AppNeta Performance Monitor if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="9500c-226">A new user is created during an attempt to access AppNeta Performance Monitor if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="9500c-227">If you need to create a user manually, contact [AppNeta Performance Monitor support team](mailto:support@appneta.com).</span><span class="sxs-lookup"><span data-stu-id="9500c-227">If you need to create a user manually, contact [AppNeta Performance Monitor support team](mailto:support@appneta.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9500c-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9500c-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="9500c-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppNeta Performance Monitor.</span><span class="sxs-lookup"><span data-stu-id="9500c-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppNeta Performance Monitor.</span></span>

![Assign the user role][200] 

<span data-ttu-id="9500c-231">**To assign Britta Simon to AppNeta Performance Monitor, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9500c-231">**To assign Britta Simon to AppNeta Performance Monitor, perform the following steps:**</span></span>

1. <span data-ttu-id="9500c-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9500c-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="9500c-234">In the applications list, select **AppNeta Performance Monitor**.</span><span class="sxs-lookup"><span data-stu-id="9500c-234">In the applications list, select **AppNeta Performance Monitor**.</span></span>

    ![The AppNeta Performance Monitor link in the Applications list](./media/appneta-tutorial/tutorial_appneta_app.png)  

3. <span data-ttu-id="9500c-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9500c-236">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="9500c-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9500c-238">Click **Add** button.</span></span> <span data-ttu-id="9500c-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9500c-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="9500c-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9500c-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9500c-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9500c-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9500c-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9500c-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9500c-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9500c-244">Test single sign-on</span></span>

<span data-ttu-id="9500c-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9500c-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9500c-246">When you click the AppNeta Performance Monitor tile in the Access Panel, you should get automatically signed-on to your AppNeta Performance Monitor application.</span><span class="sxs-lookup"><span data-stu-id="9500c-246">When you click the AppNeta Performance Monitor tile in the Access Panel, you should get automatically signed-on to your AppNeta Performance Monitor application.</span></span>
<span data-ttu-id="9500c-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9500c-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9500c-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9500c-248">Additional resources</span></span>

* [<span data-ttu-id="9500c-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9500c-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9500c-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9500c-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/appneta-tutorial/tutorial_general_01.png
[2]: ./media/appneta-tutorial/tutorial_general_02.png
[3]: ./media/appneta-tutorial/tutorial_general_03.png
[4]: ./media/appneta-tutorial/tutorial_general_04.png

[100]: ./media/appneta-tutorial/tutorial_general_100.png

[200]: ./media/appneta-tutorial/tutorial_general_200.png
[201]: ./media/appneta-tutorial/tutorial_general_201.png
[202]: ./media/appneta-tutorial/tutorial_general_202.png
[203]: ./media/appneta-tutorial/tutorial_general_203.png

